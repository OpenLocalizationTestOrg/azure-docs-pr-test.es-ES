---
title: "Tutorial: integración de Azure Active Directory con Samanage | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="2b123-103">Tutorial: integración de Azure Active Directory con Samanage</span><span class="sxs-lookup"><span data-stu-id="2b123-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="2b123-104">En este tutorial, aprenderá cómo toointegrate Samanage con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b123-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b123-105">Integración de Samanage con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="2b123-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b123-106">Puede controlar en Azure AD que tenga acceso tooSamanage</span><span class="sxs-lookup"><span data-stu-id="2b123-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="2b123-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSamanage (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b123-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2b123-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b123-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b123-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b123-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2b123-110">Prerequisites</span></span>

<span data-ttu-id="2b123-111">integración de Azure AD con Samanage tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="2b123-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="2b123-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b123-113">Una suscripción habilitada para el inicio de sesión único en Samanage</span><span class="sxs-lookup"><span data-stu-id="2b123-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b123-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="2b123-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b123-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="2b123-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b123-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2b123-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b123-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b123-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b123-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="2b123-118">Scenario description</span></span>
<span data-ttu-id="2b123-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="2b123-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b123-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="2b123-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b123-121">Agregar Samanage desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2b123-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="2b123-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="2b123-123">Agregar Samanage desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="2b123-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="2b123-124">integración de hello tooconfigure de Samanage en Azure AD, deberá tooadd Samanage de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2b123-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b123-125">**tooadd Samanage de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b123-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b123-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2b123-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2b123-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="2b123-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b123-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2b123-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="2b123-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="2b123-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="2b123-133">En el cuadro de búsqueda de hello, escriba **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="2b123-133">In hello search box, type **Samanage**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="2b123-135">En el panel de resultados de hello, seleccione **Samanage**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b123-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b123-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b123-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Samanage con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="2b123-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b123-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Samanage es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b123-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="2b123-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Samanage debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="2b123-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="2b123-141">En Samanage, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b123-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2b123-142">tooconfigure y prueba de inicio de sesión único en Azure AD con Samanage, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="2b123-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b123-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="2b123-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b123-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b123-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b123-145">**[Crear un usuario de prueba de Samanage](#creating-a-samanage-test-user)**  -toohave un equivalente de Britta Simon en Samanage que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="2b123-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b123-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2b123-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b123-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="2b123-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b123-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b123-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de Samanage.</span><span class="sxs-lookup"><span data-stu-id="2b123-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="2b123-150">**inicio de sesión único en tooconfigure Azure AD con Samanage, realice Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b123-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b123-151">En el portal de Azure, en Hola Hola **Samanage** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2b123-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="2b123-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="2b123-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="2b123-155">En hello **Samanage dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2b123-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="2b123-157">a.</span><span class="sxs-lookup"><span data-stu-id="2b123-157">a.</span></span> <span data-ttu-id="2b123-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="2b123-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="2b123-159">b.</span><span class="sxs-lookup"><span data-stu-id="2b123-159">b.</span></span> <span data-ttu-id="2b123-160">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="2b123-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b123-161">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="2b123-161">These values are not real.</span></span> <span data-ttu-id="2b123-162">Actualizar estos valores con URL de inicio de sesión real de Hola y el identificador, que se explica más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="2b123-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="2b123-163">Para más información, póngase en contacto con [equipo de soporte al cliente de Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="2b123-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="2b123-164">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2b123-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="2b123-166">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="2b123-166">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2b123-168">En hello **configuración de Samanage** sección, haga clic en **configurar Samanage** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="2b123-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2b123-169">Hola copia **dirección URL de cierre de sesión y el Id. de entidad SAML** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="2b123-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="2b123-171">En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="2b123-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="2b123-172">Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="2b123-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="2b123-173">![Panel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Panel")</span><span class="sxs-lookup"><span data-stu-id="2b123-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="2b123-174">Haga clic en **Inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="2b123-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="2b123-175">![Inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Inicio de sesión único")</span><span class="sxs-lookup"><span data-stu-id="2b123-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="2b123-176">Navegue demasiado**inicio de sesión con SAML** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="2b123-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2b123-177">![Inicio de sesión con SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Inicio de sesión con SAML")</span><span class="sxs-lookup"><span data-stu-id="2b123-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="2b123-178">a.</span><span class="sxs-lookup"><span data-stu-id="2b123-178">a.</span></span> <span data-ttu-id="2b123-179">Haga clic en **Enable Single Sign-On with SAML**(Habilitar inicio de sesión único con SAML).</span><span class="sxs-lookup"><span data-stu-id="2b123-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="2b123-180">b.</span><span class="sxs-lookup"><span data-stu-id="2b123-180">b.</span></span> <span data-ttu-id="2b123-181">Hola **dirección URL del proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b123-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="2b123-182">c.</span><span class="sxs-lookup"><span data-stu-id="2b123-182">c.</span></span> <span data-ttu-id="2b123-183">Confirmar hello **dirección URL de inicio de sesión** coincidencias hello **dirección URL de inicio de sesión** de **Samanage dominio y las direcciones URL** sección en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b123-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="2b123-184">d.</span><span class="sxs-lookup"><span data-stu-id="2b123-184">d.</span></span> <span data-ttu-id="2b123-185">Hola **Logout URL** cuadro de texto, escriba el valor de Hola de **dirección URL de cierre de sesión** que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2b123-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="2b123-186">e.</span><span class="sxs-lookup"><span data-stu-id="2b123-186">e.</span></span> <span data-ttu-id="2b123-187">Hola **emisor SAML** textbox, identificador de aplicación de tipo Hola URI establecido en el proveedor de identidad.</span><span class="sxs-lookup"><span data-stu-id="2b123-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="2b123-188">f.</span><span class="sxs-lookup"><span data-stu-id="2b123-188">f.</span></span> <span data-ttu-id="2b123-189">Abra el certificado codificado en base 64 descargado desde el portal de Azure en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **pegar su certificado a continuación de proveedor de identidades x.509** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="2b123-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="2b123-190">g.</span><span class="sxs-lookup"><span data-stu-id="2b123-190">g.</span></span> <span data-ttu-id="2b123-191">Haga clic en **Create users if they do not exist in Samanage**(Crear usuarios si no existen en Samanage).</span><span class="sxs-lookup"><span data-stu-id="2b123-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="2b123-192">h.</span><span class="sxs-lookup"><span data-stu-id="2b123-192">h.</span></span> <span data-ttu-id="2b123-193">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="2b123-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="2b123-194">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="2b123-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b123-195">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="2b123-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b123-196">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b123-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b123-197">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b123-198">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="2b123-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="2b123-200">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b123-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b123-201">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="2b123-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b123-203">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="2b123-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b123-205">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b123-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b123-207">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="2b123-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b123-209">a.</span><span class="sxs-lookup"><span data-stu-id="2b123-209">a.</span></span> <span data-ttu-id="2b123-210">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b123-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b123-211">b.</span><span class="sxs-lookup"><span data-stu-id="2b123-211">b.</span></span> <span data-ttu-id="2b123-212">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b123-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b123-213">c.</span><span class="sxs-lookup"><span data-stu-id="2b123-213">c.</span></span> <span data-ttu-id="2b123-214">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="2b123-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b123-215">d.</span><span class="sxs-lookup"><span data-stu-id="2b123-215">d.</span></span> <span data-ttu-id="2b123-216">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="2b123-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="2b123-217">Creación de un usuario de prueba en Samanage</span><span class="sxs-lookup"><span data-stu-id="2b123-217">Creating a Samanage test user</span></span>

<span data-ttu-id="2b123-218">toolog de los usuarios de Azure AD tooenable en tooSamanage, se les deben aprovisionar en Samanage.</span><span class="sxs-lookup"><span data-stu-id="2b123-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="2b123-219">En caso de hello de Samanage, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="2b123-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="2b123-220">**tooprovision una cuenta de usuario, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b123-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b123-221">Inicie sesión en su sitio de la compañía de Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="2b123-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="2b123-222">Haga clic en **Dashboard** (Panel) y seleccione **Setup** (Configuración) en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="2b123-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="2b123-223">![Instalación](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Instalación")</span><span class="sxs-lookup"><span data-stu-id="2b123-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="2b123-224">Haga clic en hello **usuarios** ficha</span><span class="sxs-lookup"><span data-stu-id="2b123-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="2b123-225">![Usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuarios")</span><span class="sxs-lookup"><span data-stu-id="2b123-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="2b123-226">Haga clic en **Nuevo usuario**.</span><span class="sxs-lookup"><span data-stu-id="2b123-226">Click **New User**.</span></span>
   
    <span data-ttu-id="2b123-227">![Nuevo usuario](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nuevo usuario")</span><span class="sxs-lookup"><span data-stu-id="2b123-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="2b123-228">Hola de tipo **nombre** hello y **dirección de correo electrónico** de una cuenta de Azure Active Directory que desee tooprovision y haga clic en **crear usuario**.</span><span class="sxs-lookup"><span data-stu-id="2b123-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="2b123-229">![Creación de usuarios](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Creación de usuarios")</span><span class="sxs-lookup"><span data-stu-id="2b123-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="2b123-230">titular de la cuenta de Hello Azure Active Directory recibirá un correo electrónico y seguir un vínculo tooconfirm su cuenta antes de activarla.</span><span class="sxs-lookup"><span data-stu-id="2b123-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="2b123-231">Puede usar cualquier otra Samanage usuario cuenta herramienta de creación o las API proporcionadas por Samanage tooprovision Azure Active Directory las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="2b123-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b123-232">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b123-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2b123-233">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="2b123-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="2b123-235">**tooassign Britta Simon tooSamanage, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="2b123-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b123-236">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="2b123-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="2b123-238">En la lista de aplicaciones de hello, seleccione **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="2b123-238">In hello applications list, select **Samanage**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="2b123-240">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b123-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="2b123-242">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="2b123-242">Click **Add** button.</span></span> <span data-ttu-id="2b123-243">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b123-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="2b123-245">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b123-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b123-246">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="2b123-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b123-247">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="2b123-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b123-248">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="2b123-248">Testing single sign-on</span></span>

<span data-ttu-id="2b123-249">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="2b123-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b123-250">Al hacer clic en icono de Samanage Hola Hola Panel de acceso, deberá obtener aplicaciones de Samanage tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="2b123-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="2b123-251">Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b123-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b123-252">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="2b123-252">Additional resources</span></span>

* [<span data-ttu-id="2b123-253">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b123-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b123-254">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b123-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

