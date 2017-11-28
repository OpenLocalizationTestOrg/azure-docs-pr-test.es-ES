---
title: "Tutorial: Integración de Azure Active Directory con Tableau Online | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y una plantilla en línea."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 590b2674270c340b4750c7b6feeaf4f0df4bf853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="86a3f-103">Tutorial: Integración de Azure Active Directory con Tableau Online</span><span class="sxs-lookup"><span data-stu-id="86a3f-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>

<span data-ttu-id="86a3f-104">En este tutorial, aprenderá cómo toointegrate Tableau Online con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="86a3f-104">In this tutorial, you learn how toointegrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="86a3f-105">Integración Tableau Online con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="86a3f-105">Integrating Tableau Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="86a3f-106">Puede controlar en Azure AD que tenga acceso tooTableau en línea</span><span class="sxs-lookup"><span data-stu-id="86a3f-106">You can control in Azure AD who has access tooTableau Online</span></span>
- <span data-ttu-id="86a3f-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooTableau en línea (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-107">You can enable your users tooautomatically get signed-on tooTableau Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="86a3f-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="86a3f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="86a3f-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="86a3f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a3f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="86a3f-110">Prerequisites</span></span>

<span data-ttu-id="86a3f-111">tooconfigure integración de Azure AD con una plantilla en línea, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="86a3f-111">tooconfigure Azure AD integration with Tableau Online, you need hello following items:</span></span>

- <span data-ttu-id="86a3f-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="86a3f-113">Una suscripción habilitada para el inicio de sesión único en Tableau Online</span><span class="sxs-lookup"><span data-stu-id="86a3f-113">A Tableau Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="86a3f-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="86a3f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="86a3f-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="86a3f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="86a3f-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="86a3f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="86a3f-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86a3f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="86a3f-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="86a3f-118">Scenario description</span></span>
<span data-ttu-id="86a3f-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="86a3f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="86a3f-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="86a3f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="86a3f-121">Agregar una plantilla en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="86a3f-121">Adding Tableau Online from hello gallery</span></span>
2. <span data-ttu-id="86a3f-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tableau-online-from-hello-gallery"></a><span data-ttu-id="86a3f-123">Agregar una plantilla en línea desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="86a3f-123">Adding Tableau Online from hello gallery</span></span>
<span data-ttu-id="86a3f-124">integración de hello tooconfigure de Tableau en línea en Azure AD, deberá tooadd Tableau en pantalla de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="86a3f-124">tooconfigure hello integration of Tableau Online into Azure AD, you need tooadd Tableau Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="86a3f-125">**tooadd Tableau en línea desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86a3f-125">**tooadd Tableau Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a3f-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="86a3f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="86a3f-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="86a3f-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="86a3f-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="86a3f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="86a3f-133">En el cuadro de búsqueda de hello, escriba **Tableau en línea**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-133">In hello search box, type **Tableau Online**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_search.png)

5. <span data-ttu-id="86a3f-135">En el panel de resultados de hello, seleccione **Tableau en línea**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="86a3f-135">In hello results panel, select **Tableau Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="86a3f-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="86a3f-138">En esta sección, configurará y probará el inicio de sesión único de Azure AD con Tableau Online con un usuario de prueba llamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a3f-138">In this section, you configure and test Azure AD single sign-on with Tableau Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="86a3f-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en una plantilla en línea es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a3f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Tableau Online is tooa user in Azure AD.</span></span> <span data-ttu-id="86a3f-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en una plantilla en línea debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="86a3f-140">In other words, a link relationship between an Azure AD user and hello related user in Tableau Online needs toobe established.</span></span>

<span data-ttu-id="86a3f-141">En línea Tableau, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a3f-141">In Tableau Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="86a3f-142">tooconfigure y prueba de inicio de sesión único en Azure AD con una plantilla en línea, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="86a3f-142">tooconfigure and test Azure AD single sign-on with Tableau Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="86a3f-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="86a3f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="86a3f-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="86a3f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="86a3f-145">**[Crear un usuario de prueba Tableau en línea](#creating-a-tableau-online-test-user)**  -toohave un equivalente de Britta Simon en una plantilla en línea que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="86a3f-145">**[Creating a Tableau Online test user](#creating-a-tableau-online-test-user)** - toohave a counterpart of Britta Simon in Tableau Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="86a3f-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="86a3f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="86a3f-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="86a3f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="86a3f-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="86a3f-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de una plantilla en línea.</span><span class="sxs-lookup"><span data-stu-id="86a3f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Tableau Online application.</span></span>

<span data-ttu-id="86a3f-150">**inicio de sesión único en tooconfigure Azure AD con una plantilla en línea realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86a3f-150">**tooconfigure Azure AD single sign-on with Tableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a3f-151">En el portal de Azure, en Hola Hola **Tableau en línea** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-151">In hello Azure portal, on hello **Tableau Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="86a3f-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="86a3f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_samlbase.png)

3. <span data-ttu-id="86a3f-155">En hello **Tableau en pantalla de dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="86a3f-155">On hello **Tableau Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_url.png)
    
    <span data-ttu-id="86a3f-157">a.</span><span class="sxs-lookup"><span data-stu-id="86a3f-157">a.</span></span> <span data-ttu-id="86a3f-158">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba la dirección URL hello:`https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="86a3f-158">In hello **Sign-on URL** textbox, type hello URL: `https://sso.online.tableau.com`</span></span>

    <span data-ttu-id="86a3f-159">b.</span><span class="sxs-lookup"><span data-stu-id="86a3f-159">b.</span></span> <span data-ttu-id="86a3f-160">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://sso.online.tableau.com/public/sp/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="86a3f-160">In hello **Identifier** textbox, type hello URL: `https://sso.online.tableau.com/public/sp/<instancename>`</span></span>

4. <span data-ttu-id="86a3f-161">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo de metadatos de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="86a3f-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_certificate.png) 

5. <span data-ttu-id="86a3f-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="86a3f-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="86a3f-165">En otra ventana del explorador, inicio de sesión tooyour aplicación Tableau en línea.</span><span class="sxs-lookup"><span data-stu-id="86a3f-165">In a different browser window, sign-on tooyour Tableau Online application.</span></span> <span data-ttu-id="86a3f-166">Vaya demasiado**configuración** y, a continuación, **autenticación**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-166">Go too**Settings** and then **Authentication**.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
    
7. <span data-ttu-id="86a3f-168">tooenable SAML, en **tipos de autenticación** sección.</span><span class="sxs-lookup"><span data-stu-id="86a3f-168">tooenable SAML, Under **Authentication Types** section.</span></span> <span data-ttu-id="86a3f-169">Comprobar hello **inicio de sesión único con SAML** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="86a3f-169">Check hello **Single sign-on with SAML** checkbox.</span></span>
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)

8. <span data-ttu-id="86a3f-171">Desplácese hacia abajo hasta la sección **Importar archivo de metadatos en Tableau Online** .</span><span class="sxs-lookup"><span data-stu-id="86a3f-171">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="86a3f-172">Haga clic en Examinar e importar el archivo de metadatos de Hola que ha descargado de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86a3f-172">Click Browse and import hello metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="86a3f-173">A continuación, haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-173">Then, click **Apply**.</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)

9. <span data-ttu-id="86a3f-175">Hola **coincide con las aserciones** sección, inserte el nombre de aserción de proveedor de identidades correspondiente de Hola para **dirección de correo electrónico**, **nombre**, y **apellidos** .</span><span class="sxs-lookup"><span data-stu-id="86a3f-175">In hello **Match assertions** section, insert hello corresponding Identity Provider assertion name for **email address**, **first name**, and **last name**.</span></span> <span data-ttu-id="86a3f-176">tooget esta información de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="86a3f-176">tooget this information from Azure AD:</span></span> 
  
    <span data-ttu-id="86a3f-177">a.</span><span class="sxs-lookup"><span data-stu-id="86a3f-177">a.</span></span> <span data-ttu-id="86a3f-178">En Hola portal de Azure, vaya hello **Tableau en línea** página de integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="86a3f-178">In hello Azure portal, go on hello **Tableau Online** application integration page.</span></span>
    
    <span data-ttu-id="86a3f-179">b.</span><span class="sxs-lookup"><span data-stu-id="86a3f-179">b.</span></span> <span data-ttu-id="86a3f-180">En la sección de atributos hello, seleccione hello **"ver y editar todos los demás atributos de usuario"** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="86a3f-180">In hello attributes section, Select hello **"view and edit all other user attributes"** checkbox.</span></span> 
    
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection.png)
      
    <span data-ttu-id="86a3f-182">c.</span><span class="sxs-lookup"><span data-stu-id="86a3f-182">c.</span></span> <span data-ttu-id="86a3f-183">Copiar valor de espacio de nombres de Hola para estos atributos: Hola givenname, correo electrónico y surname utilizando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="86a3f-183">Copy hello namespace value for these attributes: givenname, email and surname by using hello following steps:</span></span>

   ![Inicio de sesión único de Azure AD ](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
    
    <span data-ttu-id="86a3f-185">d.</span><span class="sxs-lookup"><span data-stu-id="86a3f-185">d.</span></span> <span data-ttu-id="86a3f-186">Haga clic en el valor **user.givenname**</span><span class="sxs-lookup"><span data-stu-id="86a3f-186">Click **user.givenname** value</span></span> 
    
    <span data-ttu-id="86a3f-187">e.</span><span class="sxs-lookup"><span data-stu-id="86a3f-187">e.</span></span> <span data-ttu-id="86a3f-188">Copiar valor de Hola de hello **espacio de nombres** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="86a3f-188">Copy hello value from hello **namespace** textbox.</span></span>

   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/attributesection2.png)

    <span data-ttu-id="86a3f-190">f.</span><span class="sxs-lookup"><span data-stu-id="86a3f-190">f.</span></span> <span data-ttu-id="86a3f-191">valores de espacio de nombres de hello toocopy para correo electrónico de Hola y surname siguen Hola pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="86a3f-191">toocopy hello namesapce values for hello email and surname follow hello preceding steps.</span></span>

    <span data-ttu-id="86a3f-192">g.</span><span class="sxs-lookup"><span data-stu-id="86a3f-192">g.</span></span> <span data-ttu-id="86a3f-193">Cambiar de aplicación de una plantilla en línea toohello, a continuación, establecer hello **Tableau en línea atributos** sección como sigue:</span><span class="sxs-lookup"><span data-stu-id="86a3f-193">Switch toohello Tableau Online application, then set hello **Tableau Online Attributes** section as follows:</span></span>
     * <span data-ttu-id="86a3f-194">Correo electrónico: **mail** o **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="86a3f-194">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="86a3f-195">Nombre: **givenname**</span><span class="sxs-lookup"><span data-stu-id="86a3f-195">First name: **givenname**</span></span>
     * <span data-ttu-id="86a3f-196">Apellidos: **surname**</span><span class="sxs-lookup"><span data-stu-id="86a3f-196">Last name: **surname**</span></span>
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

> [!TIP]
> <span data-ttu-id="86a3f-198">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="86a3f-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="86a3f-199">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="86a3f-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="86a3f-200">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="86a3f-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="86a3f-201">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="86a3f-202">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="86a3f-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="86a3f-204">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86a3f-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a3f-205">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="86a3f-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="86a3f-207">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="86a3f-209">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a3f-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="86a3f-211">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="86a3f-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="86a3f-213">a.</span><span class="sxs-lookup"><span data-stu-id="86a3f-213">a.</span></span> <span data-ttu-id="86a3f-214">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="86a3f-215">b.</span><span class="sxs-lookup"><span data-stu-id="86a3f-215">b.</span></span> <span data-ttu-id="86a3f-216">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="86a3f-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="86a3f-217">c.</span><span class="sxs-lookup"><span data-stu-id="86a3f-217">c.</span></span> <span data-ttu-id="86a3f-218">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="86a3f-219">d.</span><span class="sxs-lookup"><span data-stu-id="86a3f-219">d.</span></span> <span data-ttu-id="86a3f-220">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-220">Click **Create**.</span></span>
 
### <a name="creating-a-tableau-online-test-user"></a><span data-ttu-id="86a3f-221">Crear un usuario de prueba de Tableau Online</span><span class="sxs-lookup"><span data-stu-id="86a3f-221">Creating a Tableau Online test user</span></span>

<span data-ttu-id="86a3f-222">En esta sección, creará una usuaria llamada Britta Simon en Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="86a3f-222">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="86a3f-223">En **Tableau Online**, haga clic en **Settings** (Configuración) y en la sección **Authentication** (Autenticación).</span><span class="sxs-lookup"><span data-stu-id="86a3f-223">On **Tableau Online**, click **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="86a3f-224">Desplácese hacia abajo demasiado**Seleccionar usuarios** sección.</span><span class="sxs-lookup"><span data-stu-id="86a3f-224">Scroll down too**Select Users** section.</span></span> <span data-ttu-id="86a3f-225">Haga clic en **Add users** (Agregar usuarios) y en **Enter Email Addresses** (Especificar direcciones de correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="86a3f-225">Click **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="86a3f-227">Seleccione **Add users for single sign-on (SSO) authentication**[Agregar usuarios para la autenticación mediante inicio de sesión único (SSO)].</span><span class="sxs-lookup"><span data-stu-id="86a3f-227">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="86a3f-228">Hola **escribir direcciones de correo electrónico** Agregar cuadro de textobritta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="86a3f-228">In hello **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="86a3f-230">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-230">Click **Create**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="86a3f-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="86a3f-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="86a3f-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooTableau en línea.</span><span class="sxs-lookup"><span data-stu-id="86a3f-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTableau Online.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="86a3f-234">**tooassign Britta Simon tooTableau en línea, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="86a3f-234">**tooassign Britta Simon tooTableau Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="86a3f-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="86a3f-237">En la lista de aplicaciones de hello, seleccione **Tableau en línea**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-237">In hello applications list, select **Tableau Online**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_app.png) 

3. <span data-ttu-id="86a3f-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="86a3f-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-241">Click **Add** button.</span></span> <span data-ttu-id="86a3f-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="86a3f-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="86a3f-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="86a3f-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="86a3f-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="86a3f-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="86a3f-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="86a3f-247">Testing single sign-on</span></span>

<span data-ttu-id="86a3f-248">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="86a3f-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="86a3f-249">Al hacer clic en icono Tableau en línea Hola Hola Panel de acceso, deberá obtener la aplicación Tableau en línea tooyour automáticamente ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="86a3f-249">When you click hello Tableau Online tile in hello Access Panel, you should get automatically signed-on tooyour Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86a3f-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="86a3f-250">Additional resources</span></span>

* [<span data-ttu-id="86a3f-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86a3f-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="86a3f-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="86a3f-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png

