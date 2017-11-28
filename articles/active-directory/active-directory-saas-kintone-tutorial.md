---
title: "Tutorial: Integración de Azure Active Directory con Kintone | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="7d59c-103">Tutorial: Integración de Azure Active Directory con Kintone</span><span class="sxs-lookup"><span data-stu-id="7d59c-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="7d59c-104">En este tutorial, aprenderá cómo toointegrate Kintone con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7d59c-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7d59c-105">Integración Kintone con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="7d59c-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7d59c-106">Puede controlar en Azure AD que tenga acceso tooKintone</span><span class="sxs-lookup"><span data-stu-id="7d59c-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="7d59c-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooKintone (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7d59c-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7d59c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7d59c-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7d59c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d59c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7d59c-110">Prerequisites</span></span>

<span data-ttu-id="7d59c-111">integración de Azure AD con Kintone tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="7d59c-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="7d59c-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7d59c-113">Una suscripción habilitada para inicio de sesión único en Kintone</span><span class="sxs-lookup"><span data-stu-id="7d59c-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7d59c-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="7d59c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7d59c-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="7d59c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7d59c-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7d59c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7d59c-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d59c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7d59c-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="7d59c-118">Scenario description</span></span>
<span data-ttu-id="7d59c-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="7d59c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7d59c-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="7d59c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7d59c-121">Agregar Kintone desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7d59c-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="7d59c-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="7d59c-123">Agregar Kintone desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="7d59c-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="7d59c-124">integración de hello tooconfigure de Kintone en Azure AD, deberá tooadd Kintone de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="7d59c-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7d59c-125">**tooadd Kintone de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d59c-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d59c-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7d59c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7d59c-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7d59c-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="7d59c-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="7d59c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="7d59c-133">En el cuadro de búsqueda de hello, escriba **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-133">In hello search box, type **Kintone**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="7d59c-135">En el panel de resultados de hello, seleccione **Kintone**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="7d59c-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7d59c-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7d59c-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kintone con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7d59c-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7d59c-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Kintone es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d59c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="7d59c-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Kintone debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="7d59c-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="7d59c-141">En Kintone, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d59c-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7d59c-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Kintone, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="7d59c-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7d59c-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="7d59c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7d59c-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7d59c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7d59c-145">**[Crear un usuario de prueba de Kintone](#creating-a-kintone-test-user)**  -toohave un equivalente de Britta Simon en Kintone que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="7d59c-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7d59c-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7d59c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7d59c-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="7d59c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7d59c-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7d59c-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Kintone.</span><span class="sxs-lookup"><span data-stu-id="7d59c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="7d59c-150">**inicio de sesión único en Azure AD tooconfigure con Kintone, siga Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d59c-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d59c-151">En el portal de Azure, en Hola Hola **Kintone** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="7d59c-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7d59c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="7d59c-155">En hello **Kintone dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7d59c-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="7d59c-157">a.</span><span class="sxs-lookup"><span data-stu-id="7d59c-157">a.</span></span> <span data-ttu-id="7d59c-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="7d59c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="7d59c-159">b.</span><span class="sxs-lookup"><span data-stu-id="7d59c-159">b.</span></span> <span data-ttu-id="7d59c-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="7d59c-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="7d59c-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="7d59c-161">These values are not real.</span></span> <span data-ttu-id="7d59c-162">Actualizar estos valores con hello real de dirección URL de inicio de sesión y el identificador.</span><span class="sxs-lookup"><span data-stu-id="7d59c-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7d59c-163">Póngase en contacto con [equipo de soporte técnico de cliente de Kintone](https://www.kintone.com/contact/) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="7d59c-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="7d59c-164">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="7d59c-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="7d59c-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="7d59c-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7d59c-168">En hello **configuración de Kintone** sección, haga clic en **configurar Kintone** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="7d59c-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7d59c-169">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="7d59c-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="7d59c-171">En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de **Kintone** .</span><span class="sxs-lookup"><span data-stu-id="7d59c-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="7d59c-172">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="7d59c-173">![Configuración](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="7d59c-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="7d59c-174">Haga clic en **Users & System Administration** (Administración del sistema y usuarios).</span><span class="sxs-lookup"><span data-stu-id="7d59c-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="7d59c-175">![Administración de usuarios y del sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")</span><span class="sxs-lookup"><span data-stu-id="7d59c-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="7d59c-176">En **Administración del sistema \> Seguridad**, haga clic en **Inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="7d59c-177">![Inicio de sesión](./media/active-directory-saas-kintone-tutorial/ic785881.png "inicio de sesión")</span><span class="sxs-lookup"><span data-stu-id="7d59c-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="7d59c-178">Haga clic en **Habilitar autenticación SAML**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="7d59c-179">![Autenticación SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="7d59c-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="7d59c-180">En la sección autenticación SAML de hello, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7d59c-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="7d59c-181">![Autenticación SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Autenticación SAML")</span><span class="sxs-lookup"><span data-stu-id="7d59c-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="7d59c-182">a.</span><span class="sxs-lookup"><span data-stu-id="7d59c-182">a.</span></span> <span data-ttu-id="7d59c-183">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d59c-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7d59c-184">b.</span><span class="sxs-lookup"><span data-stu-id="7d59c-184">b.</span></span> <span data-ttu-id="7d59c-185">Hola **Logout URL** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d59c-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7d59c-186">c.</span><span class="sxs-lookup"><span data-stu-id="7d59c-186">c.</span></span> <span data-ttu-id="7d59c-187">Haga clic en **examinar** tooupload el certificado descargado.</span><span class="sxs-lookup"><span data-stu-id="7d59c-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="7d59c-188">d.</span><span class="sxs-lookup"><span data-stu-id="7d59c-188">d.</span></span> <span data-ttu-id="7d59c-189">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7d59c-190">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="7d59c-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7d59c-191">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="7d59c-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7d59c-192">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7d59c-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7d59c-193">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="7d59c-194">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="7d59c-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="7d59c-196">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d59c-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d59c-197">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="7d59c-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7d59c-199">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7d59c-201">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d59c-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7d59c-203">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="7d59c-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7d59c-205">a.</span><span class="sxs-lookup"><span data-stu-id="7d59c-205">a.</span></span> <span data-ttu-id="7d59c-206">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7d59c-207">b.</span><span class="sxs-lookup"><span data-stu-id="7d59c-207">b.</span></span> <span data-ttu-id="7d59c-208">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7d59c-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7d59c-209">c.</span><span class="sxs-lookup"><span data-stu-id="7d59c-209">c.</span></span> <span data-ttu-id="7d59c-210">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7d59c-211">d.</span><span class="sxs-lookup"><span data-stu-id="7d59c-211">d.</span></span> <span data-ttu-id="7d59c-212">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="7d59c-213">Creación de un usuario de prueba de Kintone</span><span class="sxs-lookup"><span data-stu-id="7d59c-213">Creating a Kintone test user</span></span>

<span data-ttu-id="7d59c-214">toolog de los usuarios de Azure AD tooenable en tooKintone, se les deben aprovisionar en Kintone.</span><span class="sxs-lookup"><span data-stu-id="7d59c-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="7d59c-215">En caso de hello de Kintone, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="7d59c-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="7d59c-216">tooprovision una cuenta de usuario, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7d59c-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="7d59c-217">Inicie sesión en tooyour **Kintone** sitio de la empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="7d59c-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="7d59c-218">Haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="7d59c-219">![Configuración](./media/active-directory-saas-kintone-tutorial/ic785879.png "Configuración")</span><span class="sxs-lookup"><span data-stu-id="7d59c-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="7d59c-220">Haga clic en **Users & System Administration** (Administración del sistema y usuarios).</span><span class="sxs-lookup"><span data-stu-id="7d59c-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="7d59c-221">![Administración de usuarios y del sistema](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")</span><span class="sxs-lookup"><span data-stu-id="7d59c-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="7d59c-222">En **Administración de usuarios** haga clic en **Departamentos y usuarios**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="7d59c-223">![Departamentos y usuarios](./media/active-directory-saas-kintone-tutorial/ic785888.png "Departamentos y usuarios")</span><span class="sxs-lookup"><span data-stu-id="7d59c-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="7d59c-224">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-224">Click **New User**.</span></span>
   
    <span data-ttu-id="7d59c-225">![Nuevos usuarios](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="7d59c-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="7d59c-226">Hola **nuevo usuario** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="7d59c-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7d59c-227">![Nuevos usuarios](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nuevos usuarios")</span><span class="sxs-lookup"><span data-stu-id="7d59c-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="7d59c-228">a.</span><span class="sxs-lookup"><span data-stu-id="7d59c-228">a.</span></span> <span data-ttu-id="7d59c-229">Escriba un **nombre para mostrar**, **nombre de inicio de sesión**, **nueva contraseña**, **Confirmar contraseña**, **dirección de correo electrónico**, y otros detalles de una cuenta válida de AAD que quiera tooprovision en hello relacionados con cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="7d59c-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="7d59c-230">b.</span><span class="sxs-lookup"><span data-stu-id="7d59c-230">b.</span></span> <span data-ttu-id="7d59c-231">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="7d59c-232">Puede usar cualquier otra Kintone usuario cuenta herramienta de creación o las API proporcionadas por Kintone tooprovision cuentas de usuario AAD.</span><span class="sxs-lookup"><span data-stu-id="7d59c-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="7d59c-233">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7d59c-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="7d59c-234">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooKintone.</span><span class="sxs-lookup"><span data-stu-id="7d59c-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="7d59c-236">**tooassign Britta Simon tooKintone, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="7d59c-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="7d59c-237">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="7d59c-239">En la lista de aplicaciones de hello, seleccione **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-239">In hello applications list, select **Kintone**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="7d59c-241">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="7d59c-243">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-243">Click **Add** button.</span></span> <span data-ttu-id="7d59c-244">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="7d59c-246">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="7d59c-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7d59c-247">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7d59c-248">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7d59c-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7d59c-249">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="7d59c-249">Testing single sign-on</span></span>

<span data-ttu-id="7d59c-250">objetivo de Hola de esta sección es tootest su configuración de inicio de sesión único de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7d59c-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7d59c-251">Al hacer clic en icono de Kintone Hola Hola Panel de acceso, deberá obtener aplicaciones de Kintone tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="7d59c-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d59c-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="7d59c-252">Additional resources</span></span>

* [<span data-ttu-id="7d59c-253">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d59c-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7d59c-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7d59c-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

