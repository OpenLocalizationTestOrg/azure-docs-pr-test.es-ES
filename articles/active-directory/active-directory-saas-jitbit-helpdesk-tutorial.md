---
title: "Tutorial: integración de Azure Active Directory con Jitbit Helpdesk | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="3653a-103">Tutorial: Integración de Azure Active Directory con Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3653a-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="3653a-104">En este tutorial, aprenderá cómo toointegrate Jitbit Helpdesk con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3653a-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3653a-105">Integración Jitbit Helpdesk con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3653a-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3653a-106">Puede controlar en Azure AD que tenga acceso tooJitbit departamento de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="3653a-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="3653a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooJitbit departamento de soporte técnico (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3653a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3653a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3653a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3653a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3653a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3653a-110">Prerequisites</span></span>

<span data-ttu-id="3653a-111">tooconfigure integración de Azure AD con Jitbit Helpdesk, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="3653a-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="3653a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3653a-113">Una suscripción habilitada para el inicio de sesión único en Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3653a-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3653a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="3653a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3653a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="3653a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3653a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3653a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3653a-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3653a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3653a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="3653a-118">Scenario description</span></span>
<span data-ttu-id="3653a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="3653a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3653a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="3653a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3653a-121">Agregar Jitbit Helpdesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3653a-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="3653a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="3653a-123">Agregar Jitbit Helpdesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="3653a-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="3653a-124">integración de hello tooconfigure de Jitbit Helpdesk en Azure AD, deberá tooadd Jitbit Helpdesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="3653a-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3653a-125">**tooadd Jitbit Helpdesk de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3653a-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3653a-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3653a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3653a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="3653a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3653a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3653a-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="3653a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3653a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="3653a-133">En el cuadro de búsqueda de hello, escriba **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="3653a-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="3653a-135">En el panel de resultados de hello, seleccione **Jitbit Helpdesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3653a-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3653a-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3653a-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Jitbit Helpdesk con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3653a-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3653a-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Jitbit Helpdesk es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3653a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="3653a-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Jitbit Helpdesk debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="3653a-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="3653a-141">En Jitbit Helpdesk, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3653a-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3653a-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Jitbit Helpdesk, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="3653a-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3653a-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="3653a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3653a-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3653a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3653a-145">**[Crear un usuario de prueba de Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user) ** -toohave un equivalente de Britta Simon en Jitbit Helpdesk que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="3653a-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3653a-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3653a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3653a-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="3653a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3653a-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3653a-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3653a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="3653a-150">**inicio de sesión único en tooconfigure Azure AD con Jitbit Helpdesk, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3653a-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3653a-151">En el portal de Azure, en Hola Hola **Jitbit Helpdesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="3653a-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="3653a-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="3653a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="3653a-155">En hello **Jitbit Helpdesk dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3653a-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="3653a-157">a.</span><span class="sxs-lookup"><span data-stu-id="3653a-157">a.</span></span> <span data-ttu-id="3653a-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="3653a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="3653a-159">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="3653a-159">This value is not real.</span></span> <span data-ttu-id="3653a-160">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="3653a-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3653a-161">Póngase en contacto con [equipo de soporte técnico de Jitbit Helpdesk cliente](https://www.jitbit.com/support/) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="3653a-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="3653a-162">b.</span><span class="sxs-lookup"><span data-stu-id="3653a-162">b.</span></span>  <span data-ttu-id="3653a-163">Hola **identificador** cuadro de texto, escriba una dirección URL como sigue:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="3653a-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="3653a-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="3653a-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="3653a-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="3653a-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3653a-168">En hello **Jitbit Helpdesk configuración** sección, haga clic en **configurar Jitbit Helpdesk** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="3653a-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3653a-169">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="3653a-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="3653a-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3653a-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="3653a-172">En la barra de herramientas de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="3653a-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="3653a-173">![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="3653a-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="3653a-174">Haga clic en **Configuración general**.</span><span class="sxs-lookup"><span data-stu-id="3653a-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="3653a-175">![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Usuarios, compañías y permisos")</span><span class="sxs-lookup"><span data-stu-id="3653a-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="3653a-176">Hola **configuración de autenticación** configuración sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3653a-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3653a-177">![Configuración de la autenticación](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Configuración de la autenticación")</span><span class="sxs-lookup"><span data-stu-id="3653a-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="3653a-178">a.</span><span class="sxs-lookup"><span data-stu-id="3653a-178">a.</span></span> <span data-ttu-id="3653a-179">Seleccione **habilitar SAML 2.0 único inicio de sesión**, toosign sesión utilizando Single Sign-On (SSO), con **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="3653a-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="3653a-180">b.</span><span class="sxs-lookup"><span data-stu-id="3653a-180">b.</span></span> <span data-ttu-id="3653a-181">Hola **dirección URL del extremo** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3653a-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="3653a-182">c.</span><span class="sxs-lookup"><span data-stu-id="3653a-182">c.</span></span> <span data-ttu-id="3653a-183">Abra su **base-64** codificado certificado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="3653a-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="3653a-184">d.</span><span class="sxs-lookup"><span data-stu-id="3653a-184">d.</span></span> <span data-ttu-id="3653a-185">Haga clic en **Guardar cambios**.</span><span class="sxs-lookup"><span data-stu-id="3653a-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="3653a-186">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="3653a-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3653a-187">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="3653a-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3653a-188">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3653a-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3653a-189">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="3653a-190">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="3653a-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="3653a-192">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3653a-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3653a-193">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="3653a-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3653a-195">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3653a-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3653a-197">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3653a-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3653a-199">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="3653a-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3653a-201">a.</span><span class="sxs-lookup"><span data-stu-id="3653a-201">a.</span></span> <span data-ttu-id="3653a-202">Hola **nombre** cuadro de texto, nombre de tipo como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3653a-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="3653a-203">b.</span><span class="sxs-lookup"><span data-stu-id="3653a-203">b.</span></span> <span data-ttu-id="3653a-204">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3653a-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3653a-205">c.</span><span class="sxs-lookup"><span data-stu-id="3653a-205">c.</span></span> <span data-ttu-id="3653a-206">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="3653a-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3653a-207">d.</span><span class="sxs-lookup"><span data-stu-id="3653a-207">d.</span></span> <span data-ttu-id="3653a-208">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3653a-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="3653a-209">Creación de un usuario de prueba de Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="3653a-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="3653a-210">En orden tooenable toolog de los usuarios de Azure AD en Jitbit Helpdesk, se les deben aprovisionar en Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3653a-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="3653a-211">En caso de hello de Jitbit Helpdesk, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="3653a-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="3653a-212">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3653a-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="3653a-213">Inicie sesión en tooyour **Jitbit Helpdesk** inquilino.</span><span class="sxs-lookup"><span data-stu-id="3653a-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="3653a-214">En el menú de hello en la parte superior de hello, haga clic en **administración**.</span><span class="sxs-lookup"><span data-stu-id="3653a-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="3653a-215">![Administración](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administración")</span><span class="sxs-lookup"><span data-stu-id="3653a-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="3653a-216">Haga clic en **Usuarios, compañías y permisos**.</span><span class="sxs-lookup"><span data-stu-id="3653a-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="3653a-217">![Usuarios, compañías y permisos](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Usuarios, compañías y permisos")</span><span class="sxs-lookup"><span data-stu-id="3653a-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="3653a-218">Haga clic en **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="3653a-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="3653a-219">![Agregar usuario](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Agregar usuario")</span><span class="sxs-lookup"><span data-stu-id="3653a-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="3653a-220">En la sección Crear hello, escriba datos Hola de cuenta de Azure AD Hola que desea tooprovision como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="3653a-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="3653a-221">![Crear](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Crear")</span><span class="sxs-lookup"><span data-stu-id="3653a-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="3653a-222">a.</span><span class="sxs-lookup"><span data-stu-id="3653a-222">a.</span></span> <span data-ttu-id="3653a-223">Hola **nombre de usuario** cuadro de texto, tipo **BrittaSimon**, nombre de usuario de hello en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3653a-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="3653a-224">b.</span><span class="sxs-lookup"><span data-stu-id="3653a-224">b.</span></span> <span data-ttu-id="3653a-225">Hola **correo electrónico** cuadro de texto, como tipo de correo electrónico del usuario de hello ** BrittaSimon@contoso.com **.</span><span class="sxs-lookup"><span data-stu-id="3653a-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="3653a-226">c.</span><span class="sxs-lookup"><span data-stu-id="3653a-226">c.</span></span> <span data-ttu-id="3653a-227">Hola **nombre** cuadro de texto Nombre de usuario de hello como tipo **Bárbara**.</span><span class="sxs-lookup"><span data-stu-id="3653a-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="3653a-228">d.</span><span class="sxs-lookup"><span data-stu-id="3653a-228">d.</span></span> <span data-ttu-id="3653a-229">Hola **Last Name** cuadro de texto, escriba Apellidos del usuario de hello como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3653a-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="3653a-230">e.</span><span class="sxs-lookup"><span data-stu-id="3653a-230">e.</span></span> <span data-ttu-id="3653a-231">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3653a-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="3653a-232">Puede usar cualquier otra Jitbit Helpdesk usuario cuenta herramienta de creación o las API proporcionadas por Jitbit Helpdesk tooprovision cuentas de usuario de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3653a-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3653a-233">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="3653a-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3653a-234">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooJitbit departamento de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="3653a-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="3653a-236">**tooassign Britta Simon tooJitbit departamento de soporte técnico, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="3653a-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="3653a-237">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="3653a-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="3653a-239">En la lista de aplicaciones de hello, seleccione **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="3653a-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="3653a-241">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3653a-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="3653a-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="3653a-243">Click **Add** button.</span></span> <span data-ttu-id="3653a-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3653a-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="3653a-246">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="3653a-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3653a-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="3653a-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3653a-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="3653a-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3653a-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="3653a-249">Testing single sign-on</span></span>

<span data-ttu-id="3653a-250">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3653a-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="3653a-251">Al hacer clic en hello Jitbit Helpdesk disponer en mosaico en el Panel de acceso de hello, deberá obtener la página de inicio de sesión de aplicación de Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="3653a-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="3653a-252">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3653a-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3653a-253">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="3653a-253">Additional resources</span></span>

* [<span data-ttu-id="3653a-254">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3653a-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3653a-255">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3653a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

