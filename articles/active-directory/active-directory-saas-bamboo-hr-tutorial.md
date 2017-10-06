---
title: "Tutorial: Integración de Azure Active Directory con BambooHR | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="66fa7-103">Tutorial: Integración de Azure Active Directory con BambooHR</span><span class="sxs-lookup"><span data-stu-id="66fa7-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="66fa7-104">En este tutorial, aprenderá cómo toointegrate BambooHR con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="66fa7-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66fa7-105">Integración de BambooHR con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="66fa7-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66fa7-106">Puede controlar en Azure AD que tenga acceso tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="66fa7-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="66fa7-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooBambooHR (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66fa7-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66fa7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="66fa7-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="66fa7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66fa7-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66fa7-110">Prerequisites</span></span>

<span data-ttu-id="66fa7-111">integración de Azure AD con BambooHR tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="66fa7-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="66fa7-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66fa7-113">Una suscripción habilitada para el inicio de sesión único en BambooHR</span><span class="sxs-lookup"><span data-stu-id="66fa7-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="66fa7-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="66fa7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="66fa7-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="66fa7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66fa7-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="66fa7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="66fa7-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="66fa7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="66fa7-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="66fa7-118">Scenario description</span></span>
<span data-ttu-id="66fa7-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="66fa7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66fa7-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="66fa7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66fa7-121">Agregar BambooHR desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66fa7-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="66fa7-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="66fa7-123">Agregar BambooHR desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="66fa7-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="66fa7-124">integración de hello tooconfigure de BambooHR en Azure AD, deberá tooadd BambooHR de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="66fa7-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66fa7-125">**tooadd BambooHR de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66fa7-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66fa7-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66fa7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66fa7-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66fa7-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="66fa7-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="66fa7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="66fa7-133">En el cuadro de búsqueda de hello, escriba **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-133">In hello search box, type **BambooHR**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="66fa7-135">En el panel de resultados de hello, seleccione **BambooHR**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="66fa7-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66fa7-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66fa7-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con BambooHR con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="66fa7-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="66fa7-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en BambooHR es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66fa7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="66fa7-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en BambooHR debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="66fa7-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="66fa7-141">En BambooHR, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66fa7-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="66fa7-142">tooconfigure y prueba de inicio de sesión único en Azure AD con BambooHR, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="66fa7-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66fa7-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="66fa7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66fa7-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="66fa7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66fa7-145">**[Crear un usuario de prueba de BambooHR](#creating-a-bamboohr-test-user)**  -toohave un equivalente de Britta Simon en BambooHR que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="66fa7-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="66fa7-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66fa7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66fa7-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="66fa7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66fa7-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66fa7-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación BambooHR.</span><span class="sxs-lookup"><span data-stu-id="66fa7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="66fa7-150">**inicio de sesión único en Azure AD tooconfigure con BambooHR, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66fa7-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="66fa7-151">En el portal de Azure, en Hola Hola **BambooHR** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="66fa7-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="66fa7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="66fa7-155">En hello **BambooHR dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66fa7-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="66fa7-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="66fa7-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="66fa7-158">Este valor no es real.</span><span class="sxs-lookup"><span data-stu-id="66fa7-158">This value is not real.</span></span> <span data-ttu-id="66fa7-159">Actualice este valor con hello dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="66fa7-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="66fa7-160">Póngase en contacto con [equipo de soporte técnico de cliente de BambooHR](https://www.bamboohr.com/contact.php) tooget este valor.</span><span class="sxs-lookup"><span data-stu-id="66fa7-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="66fa7-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="66fa7-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="66fa7-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="66fa7-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="66fa7-165">En hello **configuración de BambooHR** sección, haga clic en **configurar BambooHR** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="66fa7-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="66fa7-166">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="66fa7-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="66fa7-168">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de BambooHR.</span><span class="sxs-lookup"><span data-stu-id="66fa7-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="66fa7-169">En la página principal de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66fa7-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="66fa7-170">![Inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="66fa7-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="66fa7-171">a.</span><span class="sxs-lookup"><span data-stu-id="66fa7-171">a.</span></span> <span data-ttu-id="66fa7-172">Haga clic en **Aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="66fa7-173">b.</span><span class="sxs-lookup"><span data-stu-id="66fa7-173">b.</span></span> <span data-ttu-id="66fa7-174">En el menú de aplicaciones de Hola Hola izquierda, haga clic en **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="66fa7-175">c.</span><span class="sxs-lookup"><span data-stu-id="66fa7-175">c.</span></span> <span data-ttu-id="66fa7-176">Haga clic en **Inicio de sesión único de SAML**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="66fa7-177">Hola **SAML Single Sign-On** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="66fa7-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="66fa7-178">![Inicio de sesión único SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Inicio de sesión único SAML")</span><span class="sxs-lookup"><span data-stu-id="66fa7-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="66fa7-179">a.</span><span class="sxs-lookup"><span data-stu-id="66fa7-179">a.</span></span> <span data-ttu-id="66fa7-180">Hola pegar **SAML Single Sign-On dirección URL del servicio** valor en hello **dirección Url de inicio de sesión SSO** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="66fa7-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="66fa7-181">b.</span><span class="sxs-lookup"><span data-stu-id="66fa7-181">b.</span></span> <span data-ttu-id="66fa7-182">Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **certificado X.509** cuadro de texto</span><span class="sxs-lookup"><span data-stu-id="66fa7-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="66fa7-183">c.</span><span class="sxs-lookup"><span data-stu-id="66fa7-183">c.</span></span> <span data-ttu-id="66fa7-184">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="66fa7-185">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="66fa7-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="66fa7-186">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="66fa7-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="66fa7-187">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="66fa7-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66fa7-188">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="66fa7-189">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="66fa7-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="66fa7-191">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66fa7-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66fa7-192">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="66fa7-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66fa7-194">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66fa7-196">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="66fa7-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66fa7-198">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="66fa7-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66fa7-200">a.</span><span class="sxs-lookup"><span data-stu-id="66fa7-200">a.</span></span> <span data-ttu-id="66fa7-201">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66fa7-202">b.</span><span class="sxs-lookup"><span data-stu-id="66fa7-202">b.</span></span> <span data-ttu-id="66fa7-203">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="66fa7-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66fa7-204">c.</span><span class="sxs-lookup"><span data-stu-id="66fa7-204">c.</span></span> <span data-ttu-id="66fa7-205">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66fa7-206">d.</span><span class="sxs-lookup"><span data-stu-id="66fa7-206">d.</span></span> <span data-ttu-id="66fa7-207">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="66fa7-208">Creación de un usuario de prueba de BambooHR</span><span class="sxs-lookup"><span data-stu-id="66fa7-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="66fa7-209">toolog de los usuarios de Azure AD tooenable en tooBambooHR, se les deben aprovisionar en BambooHR.</span><span class="sxs-lookup"><span data-stu-id="66fa7-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="66fa7-210">En caso de hello de BambooHR, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="66fa7-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="66fa7-211">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66fa7-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="66fa7-212">Inicie sesión en tooyour **BambooHR** como administrador.</span><span class="sxs-lookup"><span data-stu-id="66fa7-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="66fa7-213">En la barra de herramientas de hello en la parte superior de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="66fa7-214">![Configuración](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="66fa7-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="66fa7-215">Haga clic en **Descripción general**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-215">Click **Overview**.</span></span>

4. <span data-ttu-id="66fa7-216">En el panel de navegación izquierdo de hello, vaya demasiado**seguridad \> usuarios**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="66fa7-217">Escriba el nombre de usuario de hello, contraseña y dirección de correo electrónico de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="66fa7-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="66fa7-218">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="66fa7-219">Puede usar cualquier otra BambooHR usuario cuenta herramienta de creación o las API proporcionadas por BambooHR tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="66fa7-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66fa7-220">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="66fa7-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66fa7-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooBambooHR.</span><span class="sxs-lookup"><span data-stu-id="66fa7-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="66fa7-223">**tooassign Britta Simon tooBambooHR, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="66fa7-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="66fa7-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="66fa7-226">En la lista de aplicaciones de hello, seleccione **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-226">In hello applications list, select **BambooHR**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="66fa7-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="66fa7-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-230">Click **Add** button.</span></span> <span data-ttu-id="66fa7-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="66fa7-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="66fa7-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66fa7-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66fa7-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="66fa7-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="66fa7-236">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="66fa7-236">Testing single sign-on</span></span>

<span data-ttu-id="66fa7-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="66fa7-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66fa7-238">Al hacer clic en icono de BambooHR Hola Hola Panel de acceso, deberá obtener aplicaciones de BambooHR tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="66fa7-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="66fa7-239">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="66fa7-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="66fa7-240">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="66fa7-240">Additional resources</span></span>

* [<span data-ttu-id="66fa7-241">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66fa7-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66fa7-242">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="66fa7-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

