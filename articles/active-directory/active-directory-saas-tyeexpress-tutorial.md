---
title: "Tutorial: Integración de Azure Active Directory con T&E Express | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a><span data-ttu-id="6fe99-103">Tutorial: Integración de Azure Active Directory con T&E Express</span><span class="sxs-lookup"><span data-stu-id="6fe99-103">Tutorial: Azure Active Directory integration with T&E Express</span></span>

<span data-ttu-id="6fe99-104">En este tutorial, aprenderá cómo toointegrate T & E Express con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6fe99-104">In this tutorial, you learn how toointegrate T&E Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6fe99-105">Integración de T & E Express con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="6fe99-105">Integrating T&E Express with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6fe99-106">Puede controlar en Azure AD con tooT acceso & E Express</span><span class="sxs-lookup"><span data-stu-id="6fe99-106">You can control in Azure AD who has access tooT&E Express</span></span>
- <span data-ttu-id="6fe99-107">Puede habilitar la ha iniciado sesión tooT de usuarios tooautomatically get & E Express (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-107">You can enable your users tooautomatically get signed-on tooT&E Express (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6fe99-108">Puede administrar las cuentas en una ubicación central: portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="6fe99-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="6fe99-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6fe99-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fe99-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6fe99-110">Prerequisites</span></span>

<span data-ttu-id="6fe99-111">tooconfigure integración de Azure AD con T & E Express, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="6fe99-111">tooconfigure Azure AD integration with T&E Express, you need hello following items:</span></span>

- <span data-ttu-id="6fe99-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6fe99-113">Una suscripción habilitada para inicio de sesión único en T&E Express</span><span class="sxs-lookup"><span data-stu-id="6fe99-113">A T&E Express single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6fe99-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="6fe99-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6fe99-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="6fe99-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6fe99-116">No debe usar el entorno de producción, a menos que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="6fe99-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6fe99-117">Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6fe99-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6fe99-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="6fe99-118">Scenario description</span></span>
<span data-ttu-id="6fe99-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="6fe99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6fe99-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="6fe99-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6fe99-121">Agregar T & E Express desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6fe99-121">Adding T&E Express from hello gallery</span></span>
2. <span data-ttu-id="6fe99-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-te-express-from-hello-gallery"></a><span data-ttu-id="6fe99-123">Agregar T & E Express desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="6fe99-123">Adding T&E Express from hello gallery</span></span>
<span data-ttu-id="6fe99-124">integración de hello tooconfigure de T & E Express en Azure AD, necesita tooadd T & E Express de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="6fe99-124">tooconfigure hello integration of T&E Express into Azure AD, you need tooadd T&E Express from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6fe99-125">**tooadd T & E Express desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6fe99-125">**tooadd T&E Express from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe99-126">Hola ** [Portal de administración de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6fe99-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6fe99-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6fe99-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="6fe99-131">Haga clic en **agregar** botón en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="6fe99-133">En el cuadro de búsqueda de hello, escriba **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-133">In hello search box, type **T&E Express**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. <span data-ttu-id="6fe99-135">En el panel de resultados de hello, seleccione **T & E Express**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="6fe99-135">In hello results panel, select **T&E Express**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6fe99-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6fe99-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con T&E Express con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6fe99-138">In this section, you configure and test Azure AD single sign-on with T&E Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6fe99-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en T & E Express es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fe99-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in T&E Express is tooa user in Azure AD.</span></span> <span data-ttu-id="6fe99-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en T & E Express toobe necesidades establecida.</span><span class="sxs-lookup"><span data-stu-id="6fe99-140">In other words, a link relationship between an Azure AD user and hello related user in T&E Express needs toobe established.</span></span>

<span data-ttu-id="6fe99-141">Esta relación de vínculo se establece mediante la asignación de valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** de T & E Express.</span><span class="sxs-lookup"><span data-stu-id="6fe99-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in T&E Express.</span></span>

<span data-ttu-id="6fe99-142">tooconfigure y prueba de inicio de sesión único en Azure AD con T & E Express, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="6fe99-142">tooconfigure and test Azure AD single sign-on with T&E Express, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6fe99-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="6fe99-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6fe99-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6fe99-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6fe99-145">**[Crear un usuario de prueba T & E Express](#creating-a-te-express-test-user) ** -toohave un equivalente de Britta Simon de T & E Express que está vinculado toohello Azure AD representación de ella.</span><span class="sxs-lookup"><span data-stu-id="6fe99-145">**[Creating a T&E Express test user](#creating-a-te-express-test-user)** - toohave a counterpart of Britta Simon in T&E Express that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="6fe99-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6fe99-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6fe99-147">**[Pruebas de Single Sign-On](#testing-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="6fe99-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6fe99-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6fe99-149">En esta sección, habilitar inicio de sesión único en Azure AD en el portal de administración de Azure de Hola y configurar el inicio de sesión único en la aplicación de T & E Express.</span><span class="sxs-lookup"><span data-stu-id="6fe99-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your T&E Express application.</span></span>

<span data-ttu-id="6fe99-150">**tooconfigure inicio de sesión único en Azure AD con T & E Express, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6fe99-150">**tooconfigure Azure AD single sign-on with T&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe99-151">En el portal de administración de Azure de hello, en hello **T & E Express** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-151">In hello Azure Management portal, on hello **T&E Express** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="6fe99-153">En hello **inicio de sesión único** cuadro de diálogo, como **modo** seleccione **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="6fe99-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. <span data-ttu-id="6fe99-155">En hello **T & E Express dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="6fe99-155">On hello **T&E Express Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    <span data-ttu-id="6fe99-157">a.</span><span class="sxs-lookup"><span data-stu-id="6fe99-157">a.</span></span> <span data-ttu-id="6fe99-158">Hola **identificador** cuadro de texto, valor de tipo hello como:`https://<domain>.tyeexpress.com`</span><span class="sxs-lookup"><span data-stu-id="6fe99-158">In hello **Identifier** textbox, type hello value as: `https://<domain>.tyeexpress.com`</span></span>

    <span data-ttu-id="6fe99-159">b.</span><span class="sxs-lookup"><span data-stu-id="6fe99-159">b.</span></span> <span data-ttu-id="6fe99-160">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span><span class="sxs-lookup"><span data-stu-id="6fe99-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6fe99-161">Tenga en cuenta que estos no son los valores reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="6fe99-162">Tener tooupdate estos valores con hello URL de identificador y la respuesta real.</span><span class="sxs-lookup"><span data-stu-id="6fe99-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="6fe99-163">Aquí le sugerimos toouse Hola único valor de cadena en hello identificador.</span><span class="sxs-lookup"><span data-stu-id="6fe99-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="6fe99-164">Póngase en contacto con [equipo de soporte técnico de T & E Express](http://www.tyeexpress.com/contacto.aspx) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="6fe99-164">Contact [T&E Express support team](http://www.tyeexpress.com/contacto.aspx) tooget these values.</span></span>

5. <span data-ttu-id="6fe99-165">En hello **el certificado de firma de SAML** sección, haga clic en **Metadata XML** y, a continuación, guarde el archivo XML de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="6fe99-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. <span data-ttu-id="6fe99-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="6fe99-167">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6fe99-169">inicio de sesión único en tooconfigure en **T & E rápida** aplicación rápida E sin SAML, inicio de sesión toohello T & lateral único inicio de sesión usando credenciales de administrador.</span><span class="sxs-lookup"><span data-stu-id="6fe99-169">tooconfigure single sign-on on **T&E Express** side, login toohello T&E express application without SAML single sign on using admin credentials.</span></span>

9. <span data-ttu-id="6fe99-170">En hello **administración** pestaña, haga clic en **dominio SAML** página de configuración de SAML de tooOpen Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-170">Under hello **Admin** Tab, Click on **SAML domain** tooOpen hello SAML settings page.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. <span data-ttu-id="6fe99-172">Seleccione hello **Activar(Activate)** opción de **No** demasiado**SI(Yes)**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-172">Select hello **Activar(Activate)** option from **No** too**SI(Yes)**.</span></span> <span data-ttu-id="6fe99-173">Hola **metadatos del proveedor de identidades** cuadro de texto, pegue Hola metadatos XML que tiene donwloaded desde portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6fe99-173">In hello **Identity Provider Metadata** textbox, paste hello metadata XML which you have donwloaded from Azure portal.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. <span data-ttu-id="6fe99-175">Haga clic en hello **Guardar(Save)** botón Configuración de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="6fe99-175">Click on hello **Guardar(Save)** button toosave hello settings.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6fe99-176">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="6fe99-177">objetivo de Hola de esta sección es un usuario de prueba en el portal de administración de Azure de hello llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="6fe99-177">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="6fe99-179">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6fe99-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe99-180">Hola **portal de administración de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="6fe99-180">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6fe99-182">Vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios** toodisplay lista de Hola de usuarios.</span><span class="sxs-lookup"><span data-stu-id="6fe99-182">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6fe99-184">En la parte superior de saludo del cuadro de diálogo de hello haga clic en **agregar** tooopen hello **usuario** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6fe99-184">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6fe99-186">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="6fe99-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6fe99-188">a.</span><span class="sxs-lookup"><span data-stu-id="6fe99-188">a.</span></span> <span data-ttu-id="6fe99-189">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6fe99-190">b.</span><span class="sxs-lookup"><span data-stu-id="6fe99-190">b.</span></span> <span data-ttu-id="6fe99-191">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6fe99-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6fe99-192">c.</span><span class="sxs-lookup"><span data-stu-id="6fe99-192">c.</span></span> <span data-ttu-id="6fe99-193">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="6fe99-194">d.</span><span class="sxs-lookup"><span data-stu-id="6fe99-194">d.</span></span> <span data-ttu-id="6fe99-195">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-195">Click **Create**.</span></span>
 
### <a name="creating-a-te-express-test-user"></a><span data-ttu-id="6fe99-196">Crear un usuario de prueba T & E Express</span><span class="sxs-lookup"><span data-stu-id="6fe99-196">Creating a T&E Express test user</span></span>

<span data-ttu-id="6fe99-197">En orden tooenable toolog de los usuarios de Azure AD en T & E Express, se les deben aprovisionar en T & E Express.</span><span class="sxs-lookup"><span data-stu-id="6fe99-197">In order tooenable Azure AD users toolog into T&E Express, they must be provisioned into T&E Express.</span></span>  
<span data-ttu-id="6fe99-198">En el caso de T&E Express, el aprovisionamiento es una tarea manual.</span><span class="sxs-lookup"><span data-stu-id="6fe99-198">In case of T&E Express, provisioning is a manual task.</span></span>

<span data-ttu-id="6fe99-199">**tooprovision una cuenta de usuario, realizar Hola lo siguiente:**</span><span class="sxs-lookup"><span data-stu-id="6fe99-199">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe99-200">Inicie sesión en el sitio de empresa E Express & tooyour T como administrador.</span><span class="sxs-lookup"><span data-stu-id="6fe99-200">Log in tooyour T&E Express company site as an administrator.</span></span>

2. <span data-ttu-id="6fe99-201">En la etiqueta de administración, haga clic en página principal de los usuarios tooopen Hola a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="6fe99-201">Under Admin tag, click on Users tooopen hello Users master page.</span></span>

    ![Agregar empleado](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. <span data-ttu-id="6fe99-203">En la página de inicio de hello, haga clic en ** + ** a los usuarios de tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-203">On hello home page, click on **+** tooadd hello users.</span></span>

    ![Agregar empleado](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. <span data-ttu-id="6fe99-205">Escriba todos los detalles de hello obligatorio como más frecuentes en forma de Hola y haga clic en hello guardar detalles de botón toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-205">Enter all hello mandatory details as asked in hello form and click hello save button toosave hello details.</span></span>

    ![Agregar empleado](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Agregar empleado](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="6fe99-208">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6fe99-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="6fe99-209">En esta sección, se habilita Britta Simon toouse Azure inicio de sesión único mediante la concesión de su tooT acceso & Express E.</span><span class="sxs-lookup"><span data-stu-id="6fe99-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooT&E Express.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="6fe99-211">**tooassign tooT Britta Simon & E Express, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="6fe99-211">**tooassign Britta Simon tooT&E Express, perform hello following steps:**</span></span>

1. <span data-ttu-id="6fe99-212">En el portal de administración de Azure de hello, abrir vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-212">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="6fe99-214">En la lista de aplicaciones de hello, seleccione **T & E Express**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-214">In hello applications list, select **T&E Express**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. <span data-ttu-id="6fe99-216">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="6fe99-218">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-218">Click **Add** button.</span></span> <span data-ttu-id="6fe99-219">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="6fe99-221">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="6fe99-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6fe99-222">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6fe99-223">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="6fe99-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6fe99-224">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="6fe99-224">Testing single sign-on</span></span>

<span data-ttu-id="6fe99-225">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="6fe99-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6fe99-226">Al hacer clic en hello T & Express E icono en el Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour T & E Express aplicación.</span><span class="sxs-lookup"><span data-stu-id="6fe99-226">When you click hello T&E Express tile in hello Access Panel, you should get automatically signed-on tooyour T&E Express application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6fe99-227">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="6fe99-227">Additional resources</span></span>

* [<span data-ttu-id="6fe99-228">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6fe99-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6fe99-229">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6fe99-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png

